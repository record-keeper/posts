# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-21T18:10:01.482027+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×5  [2026-10-21T18:05:18]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×25  [2026-10-21T15:13:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-10-21T13:15:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×58  [2026-10-21T10:00:22]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-21T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-21T06:00:16]
- key: `ORPHAN_SCAN|146 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-21T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-21T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=85<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-21T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-21T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-21T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=43.3% ROI=1.12 (コスト 8,600/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-21T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1833 actual=0.0000 gap=+0.1833`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-21T06:00:16]
- key: `ROI_STAT|S00: n=181 hit%=27.6% hit_CI[Bonf]=[19.2,38.0]% ROI=0.74 ROI_boot95=[0.55,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-21T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=173 hit%=35.8% hit_CI[Bonf]=[26.2,46.8]% ROI=0.98 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-21T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=85 hit%=50.6% hit_CI[Bonf]=[35.6,65.5]% ROI=0.92 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-21T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=48 hit%=35.4% ROI=0.76 (コスト 11,300/回収 8,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-21T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=41.4% ROI=1.17 (コスト 19,600/回収 23,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-21T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=61 hit%=32.8% ROI=0.85 (コスト 14,600/回収 12,440)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-21T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=52 hit%=25.0% ROI=0.78 (コスト 13,600/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-21T06:00:16]
- key: `CALIBRATION_LIVE|bt=win: n=439 pred=0.4798 actual=0.3531 error=+0.1267 (+26%) brier=0.2445 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.32MB / last modified 2026-10-21T18:09:03.892154+09:00

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
[INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-21 18:07:04,548 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-21 18:07:04,590 [INFO] predictor: Models loaded OK
2026-10-21 18:07:15,712 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=01&hd=20261021: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-21 18:07:28,201 [INFO] scraper: odds3t: 120/120 parsed
2026-10-21 18:07:29,316 [INFO] scraper: odds3f: 20/20 parsed
2026-10-21 18:07:30,438 [INFO] scraper: odds2t: 30/30 parsed
2026-10-21 18:07:30,439 [INFO] scraper: odds2f: 15/15 parsed
2026-10-21 18:07:31,549 [INFO] scraper: odds_win: 6/6 parsed
2026-10-21 18:07:31,549 [INFO] scraper: fetch_race 01/7: boats=6 odds=191/191
2026-10-21 18:07:31,552 [INFO] predictor: CALIBRATION_MODE=on
2026-10-21 18:07:31,552 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-21 18:07:31,558 [INFO] run_cycle: fetched 01/7 [scan]: 156 combos
2026-10-21 18:07:31,671 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-21 18:08:03,843 [INFO] run_cycle: === run_cycle 18:08:03 ===
2026-10-21 18:08:03,843 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-21 18:08:03,843 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-21 18:08:03,872 [INFO] predictor: Models loaded OK
2026-10-21 18:08:03,961 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-21 18:09:03,618 [INFO] run_cycle: === run_cycle 18:09:03 ===
2026-10-21 18:09:03,619 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-21 18:09:03,619 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-21 18:09:03,655 [INFO] predictor: Models loaded OK
2026-10-21 18:09:03,749 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 32
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 32
  }
]
```

## Phase別通知記録 (24h)
{'final': 11, 'result': 8, 'scan': 13}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 89
  FINAL_MISSING: 37
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 14 | 12,300 | 10,980 | -1,320 | 0.893 |
| S01_NAKAANA1 | 43 | 15 | 8,600 | 7,280 | -1,320 | 0.847 |
| S02_TETSUBAN | 14 | 9 | 2,800 | 3,780 | +980 | 1.35 |

## 直近アラート (24h・新しい順)
```
[18:05:18] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:57:31] FINAL_MISSING: {"deadline": "2026-10-21T15:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102101011526", "sid": "S00"}
[17:56:18] FINAL_MISSING: {"deadline": "2026-10-21T10:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102114051021", "sid": "S00"}
[17:53:30] FINAL_MISSING: {"deadline": "2026-10-21T14:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102116081421", "sid": "S00"}
[17:43:04] FINAL_MISSING: {"deadline": "2026-10-21T11:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102123021107", "sid": "S00"}
[17:05:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:57:03] FINAL_MISSING: {"deadline": "2026-10-21T15:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102101011526", "sid": "S00"}
[16:56:03] FINAL_MISSING: {"deadline": "2026-10-21T10:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102114051021", "sid": "S00"}
[16:53:04] FINAL_MISSING: {"deadline": "2026-10-21T14:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102116081421", "sid": "S00"}
[16:42:50] FINAL_MISSING: {"deadline": "2026-10-21T11:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102123021107", "sid": "S00"}
```

## 本日残レース: 22件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 134件 締切済
- 通知発射: scan=12 nid / final=11 nid / result=8 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 012R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.0 drift=+6.7% | 15:52:30 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5998 | 4.3 | 2.58 | 200 | scan=3.7 drift=+16.2% | 15:24:19 |
| S00 | 179R | win | 1 | 0.2290 | 18.7 | 4.28 | 300 | scan=14.2 drift=+31.7% | 13:56:19 |
| S01_NAKAANA1 | 1810R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=- drift=- | 13:13:29 |
| S02_TETSUBAN | 164R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 12:17:20 |
| S00 | 148R | win | 1 | 0.4111 | 6.1 | 2.51 | 300 | scan=5.6 drift=+8.9% | 11:53:19 |
| S00 | 147R | win | 1 | 0.5123 | 8.7 | 4.46 | 300 | scan=7.2 drift=+20.8% | 11:21:19 |
| S00 | 092R | win | 1 | 0.5174 | 12.0 | 6.21 | 300 | scan=11.2 drift=+7.1% | 10:58:44 |
| S02_TETSUBAN | 1612R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=2.7 drift=-25.9% | 16:43:30 |
| S02_TETSUBAN | 1311R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=- drift=- | 15:43:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +29.7% | -42.2% | +495.8% | 9 | 3 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 527.9s |
| **Latency** (scan→final max) | 650.9s |
| **Traffic** (notifications 24h) | 32 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 438 | 0.4792 | 0.3607 | +0.1185 | 🟡+25% | 0.2433 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 183 | 0.4408 | 0.2842 | 0.2376 | 🔴-0.17 | 0.765 |
| S01_NAKAANA1 | win | 171 | 0.4933 | 0.3626 | 0.2427 | 🔴-0.05 | 0.987 |
| S02_TETSUBAN | win | 84 | 0.5341 | 0.5238 | 0.2569 | 🔴-0.03 | 0.962 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 7 | 0.2288 | 0.2857 | 🔴-0.0570 |
| 0.30-0.50 | 154 | 0.4167 | 0.3312 | 🔴+0.0855 |
| 0.50+ | 261 | 0.5438 | 0.3908 | 🔴+0.1529 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 191 | 0.782 |
| win | <5.0 | ✅learned | 341 | 0.747 |
| win | <10.0 | ✅learned | 150 | 0.457 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-21T18:10:01.482027+09:00_