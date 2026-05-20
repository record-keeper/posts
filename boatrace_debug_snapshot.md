# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-20T13:00:01.603966+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×59 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×2 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-20T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×57  [2026-05-20T12:02:44]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-05-20T12:02:44]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×57  [2026-05-20T12:02:44]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×17  [2026-05-20T11:33:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-05-20T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=44 hit%=25.0% ROI=0.66 (コスト 13,000/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S00: n=197 hit%=26.4% hit_CI[Bonf]=[18.4,36.3]% ROI=0.91 ROI_boot95=[0.65,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=197<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=51 hit%=31.4% hit_CI[Bonf]=[16.4,51.6]% ROI=0.85 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=51<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=33 hit%=48.5% hit_CI[Bonf]=[26.3,71.2]% ROI=0.91 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=33<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-20T06:00:11]
- key: `ORPHAN_SCAN|246 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=30.6% ROI=1.30 (コスト 8,700/回収 11,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=55 hit%=29.1% ROI=0.97 (コスト 13,600/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=23 hit%=34.8% ROI=0.94 (コスト 6,000/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.02MB / last modified 2026-05-20T13:00:04.582657+09:00

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
-20 12:56:53,717 [INFO] run_cycle: fetched 11/6 [scan]: 154 combos
2026-05-20 12:56:53,907 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-20 12:57:06,209 [INFO] run_cycle: === run_cycle 12:57:06 ===
2026-05-20 12:57:06,209 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-20 12:57:06,209 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-20 12:57:06,294 [INFO] predictor: Models loaded OK
2026-05-20 12:57:06,571 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-20 12:58:05,868 [INFO] run_cycle: === run_cycle 12:58:05 ===
2026-05-20 12:58:05,868 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-20 12:58:05,868 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-20 12:58:05,935 [INFO] predictor: Models loaded OK
2026-05-20 12:58:17,727 [INFO] scraper: odds3t: 120/120 parsed
2026-05-20 12:58:18,819 [INFO] scraper: odds3f: 20/20 parsed
2026-05-20 12:58:19,926 [INFO] scraper: odds2t: 30/30 parsed
2026-05-20 12:58:19,927 [INFO] scraper: odds2f: 15/15 parsed
2026-05-20 12:58:21,048 [INFO] scraper: odds_win: 6/6 parsed
2026-05-20 12:58:21,048 [INFO] scraper: fetch_race 18/10: boats=6 odds=191/191
2026-05-20 12:58:21,059 [INFO] predictor: CALIBRATION_MODE=on
2026-05-20 12:58:21,059 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-20 12:58:21,067 [INFO] run_cycle: fetched 18/10 [scan]: 156 combos
2026-05-20 12:58:21,178 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-20 12:59:05,825 [INFO] run_cycle: === run_cycle 12:59:05 ===
2026-05-20 12:59:05,825 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-20 12:59:05,825 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-20 12:59:05,905 [INFO] predictor: Models loaded OK
2026-05-20 12:59:06,080 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 11, 'scan': 26}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 59
  ANOMALY_SCRAPER_FAILURE_BURST: 46
  KS_ODDS_DRIFT: 43
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  CIRCUIT_BREAKER_TRIP: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 11 | 9,600 | 12,780 | +3,180 | 1.331 |
| S01_NAKAANA1 | 26 | 4 | 5,200 | 4,200 | -1,000 | 0.808 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 2,280 | -1,120 | 0.671 |

## 直近アラート (24h・新しい順)
```
[12:53:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.41}
[12:45:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.406}
[12:40:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.413}
[12:31:30] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.42}
[12:16:22] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.43}
[12:12:37] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.418}
[12:10:40] FINAL_MISSING: {"deadline": "2026-05-20T11:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052005011140", "sid": "S00"}
[12:02:43] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:43] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:55:53] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.415}
```

## 本日残レース: 91件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 53件 締切済
- 通知発射: scan=9 nid / final=7 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 175R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=3.8 drift=-18.4% | 12:53:21 |
| S00 | 164R | win | 1 | 0.4111 | 7.9 | 3.25 | 300 | scan=6.0 drift=+31.7% | 12:31:20 |
| S00 | 149R | win | 1 | 0.5334 | 4.5 | 2.40 | 300 | scan=7.0 drift=-35.7% | 12:12:22 |
| S00 | 148R | win | 1 | 0.5123 | 4.0 | 2.05 | 300 | scan=6.0 drift=-33.3% | 11:40:35 |
| S00 | 162R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=6.3 drift=+6.3% | 11:27:30 |
| S02_TETSUBAN | 211R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.3 drift=-4.3% | 10:45:32 |
| S02_TETSUBAN | 207R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=2.2 drift=+13.6% | 20:22:21 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 16:30:24 |
| S01_NAKAANA1 | 088R | win | 1 | 0.5174 | 4.7 | 2.43 | 200 | scan=- drift=- | 13:45:22 |
| S00 | 088R | win | 1 | 0.5174 | 4.7 | 2.43 | 300 | scan=- drift=- | 13:45:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | -3.0% | -76.3% | +148.9% | 18 | 9 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 469.2s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 283 | 0.4540 | 0.3004 | +0.1537 | 🟡+34% | 0.2306 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 198 | 0.4351 | 0.2677 | 0.2260 | 🔴-0.15 | 0.925 |
| S01_NAKAANA1 | win | 51 | 0.4904 | 0.3137 | 0.2346 | 🔴-0.09 | 0.855 |
| S02_TETSUBAN | win | 34 | 0.5095 | 0.4706 | 0.2507 | 🔴-0.01 | 0.879 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 127 | 0.4239 | 0.2362 | 🔴+0.1877 |
| 0.50+ | 130 | 0.5396 | 0.3769 | 🔴+0.1627 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 16 | 0.775 |
| win | <5.0 | ✅learned | 32 | 0.831 |
| win | <10.0 | ✅learned | 26 | 0.556 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-20T13:00:01.603966+09:00_