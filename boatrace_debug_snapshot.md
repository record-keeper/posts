# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-06T20:50:01.446004+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×43  [2026-10-06T20:07:25]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-10-06T20:07:25]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-06T19:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×13  [2026-10-06T16:35:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×17  [2026-10-06T16:03:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-10-06T16:02:20]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×16  [2026-10-06T15:02:34]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-06T13:30:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S00: n=167 hit%=22.8% hit_CI[Bonf]=[14.8,33.3]% ROI=0.63 ROI_boot95=[0.43,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=30.5% hit_CI[Bonf]=[21.4,41.5]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=48.2% hit_CI[Bonf]=[33.3,63.5]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-06T06:00:21]
- key: `ORPHAN_SCAN|174 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=40.6% ROI=1.12 (コスト 8,900/回収 9,950)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=25.5% ROI=0.69 (コスト 12,000/回収 8,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=28.1% ROI=0.75 (コスト 20,100/回収 15,050)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=44 hit%=36.4% ROI=0.81 (コスト 10,200/回収 8,240)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.11MB / last modified 2026-10-06T20:49:04.987960+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
ault=5000
2026-10-06 20:46:04,356 [INFO] predictor: Models loaded OK
2026-10-06 20:46:16,763 [INFO] scraper: odds3t: 120/120 parsed
2026-10-06 20:46:17,840 [INFO] scraper: odds3f: 20/20 parsed
2026-10-06 20:46:18,948 [INFO] scraper: odds2t: 30/30 parsed
2026-10-06 20:46:18,950 [INFO] scraper: odds2f: 13/15 parsed
2026-10-06 20:46:20,056 [INFO] scraper: odds_win: 4/6 parsed
2026-10-06 20:46:20,056 [INFO] scraper: fetch_race 20/7: boats=6 odds=187/191
2026-10-06 20:46:20,060 [INFO] predictor: CALIBRATION_MODE=on
2026-10-06 20:46:20,060 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-06 20:46:20,065 [INFO] run_cycle: fetched 20/7 [scan]: 154 combos
2026-10-06 20:46:20,183 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-06 20:47:04,718 [INFO] run_cycle: === run_cycle 20:47:04 ===
2026-10-06 20:47:04,718 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-06 20:47:04,718 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-06 20:47:04,765 [INFO] predictor: Models loaded OK
2026-10-06 20:47:04,868 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-06 20:48:03,949 [INFO] run_cycle: === run_cycle 20:48:03 ===
2026-10-06 20:48:03,949 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-06 20:48:03,949 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-06 20:48:03,995 [INFO] predictor: Models loaded OK
2026-10-06 20:48:04,087 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-06 20:49:04,550 [INFO] run_cycle: === run_cycle 20:49:04 ===
2026-10-06 20:49:04,550 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-06 20:49:04,550 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-06 20:49:04,584 [INFO] predictor: Models loaded OK
2026-10-06 20:49:04,586 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 15, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 154
  FINAL_MISSING: 61
  ANOMALY_SCAN_FINAL_RATIO: 28
  CIRCUIT_BREAKER_NO_ACTION: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 10
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 18 | 15,300 | 14,370 | -930 | 0.939 |
| S01_NAKAANA1 | 46 | 20 | 9,200 | 14,280 | +5,080 | 1.552 |
| S02_TETSUBAN | 16 | 7 | 3,200 | 2,140 | -1,060 | 0.669 |

## 直近アラート (24h・新しい順)
```
[20:46:20] FINAL_MISSING: {"deadline": "2026-10-06T13:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100605061312", "sid": "S01_NAKAANA1"}
[20:34:04] FINAL_MISSING: {"deadline": "2026-10-06T10:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100611021058", "sid": "S00"}
[20:27:03] FINAL_MISSING: {"deadline": "2026-10-06T11:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100611041154", "sid": "S00"}
[20:18:30] FINAL_MISSING: {"deadline": "2026-10-06T10:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100613011043", "sid": "S00"}
[20:07:25] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[20:07:25] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[20:04:26] FINAL_MISSING: {"deadline": "2026-10-06T18:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100620021834", "sid": "S00"}
[19:53:25] FINAL_MISSING: {"deadline": "2026-10-06T12:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100602041219", "sid": "S00"}
[19:45:30] FINAL_MISSING: {"deadline": "2026-10-06T13:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100605061312", "sid": "S01_NAKAANA1"}
[19:34:04] FINAL_MISSING: {"deadline": "2026-10-06T10:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100611021058", "sid": "S00"}
```

## 本日残レース: 6件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 150件 締切済
- 通知発射: scan=22 nid / final=24 nid / result=13 nid
- predictions: 13 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 204R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 19:27:18 |
| S01_NAKAANA1 | 202R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.3 drift=+0.0% | 18:31:30 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5990 | 3.9 | 2.34 | 200 | scan=3.1 drift=+25.8% | 18:05:19 |
| S01_NAKAANA1 | 0212R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.1 drift=+0.0% | 16:27:19 |
| S02_TETSUBAN | 1312R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.7 drift=-7.4% | 16:22:18 |
| S00 | 1111R | win | 1 | 0.5174 | 17.4 | 9.00 | 300 | scan=- drift=- | 15:30:21 |
| S02_TETSUBAN | 0510R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 15:18:18 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5476 | 3.0 | 1.64 | 200 | scan=3.3 drift=-9.1% | 14:20:22 |
| S02_TETSUBAN | 138R | win | 1 | 0.5476 | 2.4 | 1.31 | 200 | scan=- drift=- | 14:07:19 |
| S00 | 137R | win | 1 | 0.5123 | 13.6 | 6.97 | 300 | scan=- drift=- | 13:39:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 75 | +6.7% | -76.2% | +169.2% | 24 | 11 | 55 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 463.1s |
| **Latency** (scan→final max) | 611.7s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 413 | 0.4789 | 0.3123 | +0.1665 | 🟡+35% | 0.2498 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4491 | 0.2275 | 0.2466 | 🔴-0.40 | 0.598 |
| S01_NAKAANA1 | win | 166 | 0.4882 | 0.3133 | 0.2502 | 🔴-0.16 | 1.019 |
| S02_TETSUBAN | win | 80 | 0.5216 | 0.4875 | 0.2555 | 🔴-0.02 | 0.833 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 163 | 0.4197 | 0.2945 | 🔴+0.1252 |
| 0.50+ | 234 | 0.5433 | 0.3291 | 🔴+0.2142 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 170 | 0.767 |
| win | <5.0 | ✅learned | 301 | 0.764 |
| win | <10.0 | ✅learned | 136 | 0.457 |
| win | <20.0 | ✅learned | 38 | 0.243 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-06T20:50:01.446004+09:00_